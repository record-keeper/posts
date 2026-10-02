# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-02T11:50:01.481405+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×27 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×23  [2026-10-02T11:26:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×45  [2026-10-02T11:04:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×45  [2026-10-02T11:04:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-10-02T11:04:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-10-02T11:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×52  [2026-10-02T10:56:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-02T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-10-02T06:00:26]
- key: `ORPHAN_SCAN|182 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-02T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-02T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-02T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=159<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-02T06:00:26]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-02T06:00:26]
- key: `ROI_STAT|S00: n=169 hit%=21.3% hit_CI[Bonf]=[13.7,31.6]% ROI=0.61 ROI_boot95=[0.41,0.84]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-02T06:00:26]
- key: `ROI_STAT|S01_NAKAANA1: n=159 hit%=25.8% hit_CI[Bonf]=[17.2,36.8]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-02T06:00:26]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=48.8% hit_CI[Bonf]=[33.5,64.2]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=35.5% ROI=1.00 (コスト 8,700/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=24.4% ROI=0.65 (コスト 10,500/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=26.7% ROI=0.79 (コスト 20,900/回収 16,520)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=43 hit%=27.9% ROI=0.50 (コスト 9,700/回収 4,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift ≥+30%: n=43 hit%=9.3% ROI=0.18 (コスト 11,300/回収 2,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.76MB / last modified 2026-10-02T11:49:38.402948+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
:19,736 [INFO] run_cycle: fetched 06/2 [final]: 155 combos
2026-10-02 11:49:21,612 [INFO] race_id: notif: nid=2026100206021152 sid=S01_NAKAANA1 phase=final rank=B
2026-10-02 11:49:21,938 [INFO] notifier: Discord notify OK (status=204)
2026-10-02 11:49:23,053 [INFO] notifier: Discord notify OK (status=204)
2026-10-02 11:49:23,348 [INFO] run_cycle: FINAL S01_NAKAANA1 浜名湖2R B
2026-10-02 11:49:26,829 [INFO] scraper: odds3t: 120/120 parsed
2026-10-02 11:49:27,950 [INFO] scraper: odds3f: 20/20 parsed
2026-10-02 11:49:29,051 [INFO] scraper: odds2t: 30/30 parsed
2026-10-02 11:49:29,052 [INFO] scraper: odds2f: 15/15 parsed
2026-10-02 11:49:30,148 [INFO] scraper: odds_win: 6/6 parsed
2026-10-02 11:49:30,149 [INFO] scraper: fetch_race 04/3: boats=6 odds=191/191
2026-10-02 11:49:30,151 [INFO] predictor: CALIBRATION_MODE=on
2026-10-02 11:49:30,151 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-02 11:49:30,155 [INFO] run_cycle: fetched 04/3 [scan]: 156 combos
2026-10-02 11:49:33,954 [INFO] scraper: odds3t: 120/120 parsed
2026-10-02 11:49:35,066 [INFO] scraper: odds3f: 20/20 parsed
2026-10-02 11:49:36,145 [INFO] scraper: odds2t: 27/30 parsed
2026-10-02 11:49:36,147 [INFO] scraper: odds2f: 14/15 parsed
2026-10-02 11:49:37,222 [INFO] scraper: odds_win: 5/6 parsed
2026-10-02 11:49:37,222 [INFO] scraper: fetch_race 13/4: boats=6 odds=186/191
2026-10-02 11:49:37,225 [INFO] predictor: CALIBRATION_MODE=on
2026-10-02 11:49:37,225 [INFO] predictor: combos: {'win': 5, '2t': 27, '3t': 120}
2026-10-02 11:49:37,229 [INFO] run_cycle: fetched 13/4 [scan]: 152 combos
2026-10-02 11:49:37,392 [INFO] run_cycle: run_cycle done: 1 notifications
2026-10-02 11:50:06,866 [INFO] run_cycle: === run_cycle 11:50:06 ===
2026-10-02 11:50:06,866 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-02 11:50:06,866 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-02 11:50:06,920 [INFO] predictor: Models loaded OK

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 91
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 91
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 22, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 116
  FINAL_MISSING: 72
  CIRCUIT_BREAKER_NO_ACTION: 29
  CIRCUIT_BREAKER_TRIP: 27
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 9 | 14,100 | 6,660 | -7,440 | 0.472 |
| S01_NAKAANA1 | 47 | 13 | 9,400 | 8,180 | -1,220 | 0.87 |
| S02_TETSUBAN | 21 | 12 | 4,200 | 3,980 | -220 | 0.948 |

## 直近アラート (24h・新しい順)
```
[11:49:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.195, "baseline_mean": 0.795, "baseline_stdev": 0.057, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -3.39}
[11:48:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1111}
[11:47:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1116}
[11:44:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1124}
[11:43:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1123}
[11:42:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1119}
[11:42:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.395, "baseline_mean": 0.795, "baseline_stdev": 0.057, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.4, "today_scan_count": 5, "z_score": -6.88}
[11:41:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1098}
[11:40:23] FINAL_MISSING: {"deadline": "2026-10-02T09:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100223020909", "sid": "S00"}
[11:40:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1100}
```

## 本日残レース: 132件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 36件 締切済
- 通知発射: scan=5 nid / final=7 nid / result=2 nid
- predictions: 6 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 062R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=3.1 drift=+6.5% | 11:49:19 |
| S01_NAKAANA1 | 148R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:45:45 |
| S00 | 187R | win | 1 | 0.5334 | 4.7 | 2.51 | 300 | scan=- drift=- | 11:35:20 |
| S00 | 222R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=6.0 drift=-5.0% | 11:33:20 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=- drift=- | 10:52:20 |
| S01_NAKAANA1 | 234R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=- drift=- | 09:58:21 |
| S00 | 197R | win | 1 | 0.2267 | 6.0 | 1.36 | 300 | scan=4.5 drift=+33.3% | 18:12:22 |
| S00 | 076R | win | 1 | 0.4111 | 6.6 | 2.71 | 300 | scan=15.7 drift=-58.0% | 17:33:33 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.0 drift=+36.7% | 16:41:19 |
| S00 | 153R | win | 1 | 0.5174 | 14.6 | 7.55 | 300 | scan=24.7 drift=-40.9% | 16:08:28 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 75 | +7.7% | -76.2% | +357.1% | 25 | 10 | 52 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 467.3s |
| **Latency** (scan→final max) | 662.0s |
| **Traffic** (notifications 24h) | 91 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4782 | 0.2836 | +0.1946 | 🟡+41% | 0.2459 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4449 | 0.2143 | 0.2415 | 🔴-0.43 | 0.615 |
| S01_NAKAANA1 | win | 161 | 0.4908 | 0.2547 | 0.2470 | 🔴-0.30 | 0.784 |
| S02_TETSUBAN | win | 80 | 0.5227 | 0.4875 | 0.2532 | 🔴-0.01 | 0.825 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 153 | 0.4156 | 0.2353 | 🔴+0.1803 |
| 0.50+ | 239 | 0.5428 | 0.3180 | 🔴+0.2248 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 165 | 0.77 |
| win | <5.0 | ✅learned | 283 | 0.757 |
| win | <10.0 | ✅learned | 130 | 0.461 |
| win | <20.0 | ✅learned | 34 | 0.237 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-02T11:50:01.481405+09:00_