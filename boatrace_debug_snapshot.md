# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-19T13:00:01.699220+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×53 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×53 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-19T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-19T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×19  [2026-07-19T12:41:32]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×39  [2026-07-19T12:09:43]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×114  [2026-07-19T12:01:58]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×114  [2026-07-19T12:01:58]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-07-19T12:01:58]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-07-19T09:00:20]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-19T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-19T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-19T06:00:05]
- key: `ROI_STAT|S00: n=186 hit%=26.9% hit_CI[Bonf]=[18.6,37.1]% ROI=0.68 ROI_boot95=[0.51,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-19T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S00: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-19T06:00:05]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=29.5% hit_CI[Bonf]=[20.5,40.5]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-19T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-19T06:00:05]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=45.2% hit_CI[Bonf]=[29.8,61.6]% ROI=0.93 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-19T06:00:05]
- key: `ORPHAN_SCAN|163 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-19T06:00:05]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=26.5% ROI=0.66 (コスト 9,800/回収 6,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-19T06:00:05]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=48 hit%=33.3% ROI=0.78 (コスト 11,700/回収 9,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-19T06:00:05]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=33.7% ROI=0.81 (コスト 20,300/回収 16,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-19T06:00:05]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=33 hit%=27.3% ROI=0.54 (コスト 8,000/回収 4,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.07MB / last modified 2026-07-19T13:00:03.348722+09:00

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
:58:37,821 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-19 12:59:03,520 [INFO] run_cycle: === run_cycle 12:59:03 ===
2026-07-19 12:59:03,520 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-19 12:59:03,520 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-19 12:59:03,565 [INFO] predictor: Models loaded OK
2026-07-19 12:59:14,898 [INFO] scraper: odds3t: 120/120 parsed
2026-07-19 12:59:15,996 [INFO] scraper: odds3f: 20/20 parsed
2026-07-19 12:59:17,100 [INFO] scraper: odds2t: 30/30 parsed
2026-07-19 12:59:17,101 [INFO] scraper: odds2f: 13/15 parsed
2026-07-19 12:59:18,198 [INFO] scraper: odds_win: 6/6 parsed
2026-07-19 12:59:18,198 [INFO] scraper: fetch_race 18/10: boats=6 odds=189/191
2026-07-19 12:59:18,202 [INFO] predictor: CALIBRATION_MODE=on
2026-07-19 12:59:18,202 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-19 12:59:18,207 [INFO] run_cycle: fetched 18/10 [scan]: 156 combos
2026-07-19 12:59:21,740 [INFO] scraper: odds3t: 120/120 parsed
2026-07-19 12:59:22,836 [INFO] scraper: odds3f: 20/20 parsed
2026-07-19 12:59:23,909 [INFO] scraper: odds2t: 30/30 parsed
2026-07-19 12:59:23,911 [INFO] scraper: odds2f: 15/15 parsed
2026-07-19 12:59:25,008 [INFO] scraper: odds_win: 5/6 parsed
2026-07-19 12:59:25,008 [INFO] scraper: fetch_race 09/6: boats=6 odds=190/191
2026-07-19 12:59:25,011 [INFO] predictor: CALIBRATION_MODE=on
2026-07-19 12:59:25,011 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-19 12:59:25,015 [INFO] run_cycle: fetched 09/6 [scan]: 155 combos
2026-07-19 12:59:25,049 [INFO] race_id: notif: nid=2026071909061309 sid=S02_TETSUBAN phase=scan rank=B
2026-07-19 12:59:25,428 [INFO] notifier: Discord notify OK (status=204)
2026-07-19 12:59:26,039 [INFO] notifier: Discord notify OK (status=204)
2026-07-19 12:59:26,062 [INFO] run_cycle: SCAN S02_TETSUBAN 津6R B
2026-07-19 12:59:26,278 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 86
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 86
  }
]
```

## Phase別通知記録 (24h)
{'final': 32, 'result': 23, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 169
  FINAL_MISSING: 55
  CIRCUIT_BREAKER_TRIP: 53
  CIRCUIT_BREAKER_NO_ACTION: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 9 | 12,900 | 8,010 | -4,890 | 0.621 |
| S01_NAKAANA1 | 38 | 9 | 7,600 | 4,800 | -2,800 | 0.632 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 3,440 | -360 | 0.905 |

## 直近アラート (24h・新しい順)
```
[12:59:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1363}
[12:59:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.32, "baseline_mean": 0.82, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 10, "z_score": -4.29}
[12:58:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1349}
[12:57:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1373}
[12:56:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1374}
[12:55:54] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1348}
[12:54:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1370}
[12:52:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1371}
[12:51:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1369}
[12:50:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1384}
```

## 本日残レース: 127件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 65件 締切済
- 通知発射: scan=10 nid / final=10 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 024R | win | 1 | 0.5334 | 4.2 | 2.24 | 200 | scan=- drift=- | 12:11:30 |
| S02_TETSUBAN | 218R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 11:44:19 |
| S01_NAKAANA1 | 093R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=- drift=- | 11:33:19 |
| S01_NAKAANA1 | 107R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=- drift=- | 11:18:30 |
| S00 | 107R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 11:18:29 |
| S00 | 106R | win | 1 | 0.1656 | 14.0 | 2.32 | 300 | scan=- drift=- | 10:48:42 |
| S00 | 171R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=- drift=- | 10:40:32 |
| S02_TETSUBAN | 091R | win | 1 | 0.4941 | 2.2 | 1.09 | 200 | scan=- drift=- | 10:30:20 |
| S02_TETSUBAN | 0710R | win | 1 | 0.5123 | 2.4 | 1.23 | 200 | scan=2.6 drift=-7.7% | 19:32:18 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=- drift=- | 16:49:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +6.3% | -64.6% | +231.3% | 16 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 476.8s |
| **Latency** (scan→final max) | 662.7s |
| **Traffic** (notifications 24h) | 86 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 428 | 0.4671 | 0.3061 | +0.1611 | 🟡+34% | 0.2375 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 188 | 0.4265 | 0.2660 | 0.2278 | 🔴-0.17 | 0.679 |
| S01_NAKAANA1 | win | 166 | 0.4801 | 0.2892 | 0.2392 | 🔴-0.16 | 0.748 |
| S02_TETSUBAN | win | 74 | 0.5413 | 0.4459 | 0.2586 | 🔴-0.05 | 0.922 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1762 | 0.5000 | 🔴-0.3238 |
| 0.20-0.30 | 16 | 0.2269 | 0.2500 | ✅-0.0231 |
| 0.30-0.50 | 165 | 0.4165 | 0.2606 | 🔴+0.1558 |
| 0.50+ | 231 | 0.5425 | 0.3420 | 🔴+0.2006 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 77 | 0.81 |
| win | <5.0 | ✅learned | 147 | 0.706 |
| win | <10.0 | ✅learned | 75 | 0.466 |
| win | <20.0 | ✅learned | 24 | 0.222 |
| win | <50.0 | ⚠️fallback | 4 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-19T13:00:01.699220+09:00_