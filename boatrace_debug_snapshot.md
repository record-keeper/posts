# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-30T13:50:01.386292+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×29 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×88 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-30T13:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CIRCUIT_BREAKER_TRIP  ×28  [2026-10-30T13:10:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×28  [2026-10-30T13:10:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×14  [2026-10-30T13:10:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×16  [2026-10-30T13:01:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×16  [2026-10-30T13:01:19]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-30T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-30T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-30T13:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×18  [2026-10-30T12:53:52]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-30T12:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-10-30T10:30:09]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-30T09:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ORPHAN_SCAN  ×1  [2026-10-30T06:00:50]
- key: `ORPHAN_SCAN|152 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-30T06:00:50]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-30T06:00:50]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1854 actual=0.0000 gap=+0.1854`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-30T06:00:50]
- key: `DRIFT_BUCKET|drift ≥+30%: n=51 hit%=25.5% ROI=0.83 (コスト 13,500/回収 11,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-30T06:00:50]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2288 actual=0.2000 gap=+0.0288`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-30T06:00:50]
- key: `ROI_STAT|S00: n=191 hit%=31.4% hit_CI[Bonf]=[22.7,41.7]% ROI=0.85 ROI_boot95=[0.65,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-30T06:00:50]
- key: `INSUFFICIENT_SAMPLE|S00: n=191<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.17MB / last modified 2026-10-30T13:47:52.171255+09:00

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
dds2t: 30/30 parsed
2026-10-30 13:47:41,579 [INFO] scraper: odds2f: 15/15 parsed
2026-10-30 13:47:50,682 [INFO] scraper: odds_win: 6/6 parsed
2026-10-30 13:47:50,683 [INFO] scraper: fetch_race 08/8: boats=6 odds=191/191
2026-10-30 13:47:50,686 [INFO] predictor: CALIBRATION_MODE=on
2026-10-30 13:47:50,686 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-30 13:47:50,690 [INFO] run_cycle: fetched 08/8 [final]: 156 combos
2026-10-30 13:47:50,990 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-30 13:48:04,597 [INFO] run_cycle: === run_cycle 13:48:04 ===
2026-10-30 13:48:04,597 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-30 13:48:04,597 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-30 13:48:04,627 [INFO] predictor: Models loaded OK
2026-10-30 13:48:15,668 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=18&hd=20261030: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-30 13:48:26,727 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=18&hd=20261030: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-30 13:48:59,461 [INFO] scraper: odds3t: 120/120 parsed
2026-10-30 13:49:09,547 [INFO] scraper: odds3f: 20/20 parsed
2026-10-30 13:49:19,640 [INFO] scraper: odds2t: 30/30 parsed
2026-10-30 13:49:19,642 [INFO] scraper: odds2f: 15/15 parsed
2026-10-30 13:49:28,744 [INFO] scraper: odds_win: 3/6 parsed
2026-10-30 13:49:28,745 [INFO] scraper: fetch_race 18/11: boats=6 odds=188/191
2026-10-30 13:49:28,748 [INFO] predictor: CALIBRATION_MODE=on
2026-10-30 13:49:28,748 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-10-30 13:49:28,753 [INFO] run_cycle: fetched 18/11 [final]: 153 combos
2026-10-30 13:49:58,343 [INFO] scraper: odds3t: 120/120 parsed

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
    "c": 34
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 34
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 7, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  FINAL_MISSING: 88
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 16
  ANOMALY_SCAN_FINAL_RATIO: 12
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 13 | 13,800 | 9,030 | -4,770 | 0.654 |
| S01_NAKAANA1 | 41 | 11 | 8,200 | 5,600 | -2,600 | 0.683 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 4,100 | +1,700 | 1.708 |

## 直近アラート (24h・新しい順)
```
[13:47:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[13:45:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[13:42:25] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 9030, "roi_7d": 0.654, "sid": "S00"}
[13:42:25] FINAL_MISSING: {"deadline": "2026-10-30T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103023081206", "sid": "S01_NAKAANA1"}
[13:42:25] FINAL_MISSING: {"deadline": "2026-10-30T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103023081206", "sid": "S00"}
[13:42:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 494}
[13:42:25] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.511, "baseline_mean": 0.811, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.3, "today_scan_count": 10, "z_score": -4.67}
[13:42:25] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 9.3, "baseline_n_days": 7, "baseline_stdev": 3.6, "hour": 13, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 2, "z_score": -2.0}
[13:37:48] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 5600, "roi_7d": 0.683, "sid": "S01_NAKAANA1"}
[13:37:48] FINAL_MISSING: {"deadline": "2026-10-30T11:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103023061101", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 76件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 68件 締切済
- 通知発射: scan=10 nid / final=4 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 067R | win | 1 | 0.5735 | 8.3 | 4.76 | 300 | scan=18.2 drift=-54.4% | 13:39:39 |
| S02_TETSUBAN | 031R | win | 1 | 0.6031 | 2.2 | 1.33 | 200 | scan=- drift=- | 10:57:28 |
| S01_NAKAANA1 | 075R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 17:09:25 |
| S01_NAKAANA1 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 200 | scan=4.5 drift=-6.7% | 16:38:51 |
| S00 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 300 | scan=4.5 drift=-6.7% | 16:38:48 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 16:15:38 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5990 | 3.7 | 2.22 | 200 | scan=- drift=- | 14:00:01 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=3.1 drift=+54.8% | 13:24:39 |
| S00 | 145R | win | 1 | 0.5123 | 13.5 | 6.92 | 300 | scan=26.0 drift=-48.1% | 10:25:16 |
| S01_NAKAANA1 | 144R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=3.3 drift=+6.1% | 09:51:37 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +6.2% | -77.4% | +111.7% | 17 | 6 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 426.4s |
| **Latency** (scan→final max) | 662.1s |
| **Traffic** (notifications 24h) | 34 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 444 | 0.4792 | 0.3491 | +0.1301 | 🟡+27% | 0.2415 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 187 | 0.4440 | 0.3155 | 0.2352 | 🔴-0.09 | 0.844 |
| S01_NAKAANA1 | win | 187 | 0.4884 | 0.3369 | 0.2404 | 🔴-0.08 | 0.885 |
| S02_TETSUBAN | win | 70 | 0.5487 | 0.4714 | 0.2611 | 🔴-0.05 | 1.047 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1854 | 0.0000 | 🔴+0.1854 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 157 | 0.4134 | 0.3185 | 🔴+0.0949 |
| 0.50+ | 264 | 0.5438 | 0.3826 | 🔴+0.1612 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 358 | 0.741 |
| win | <10.0 | ✅learned | 156 | 0.45 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-30T13:50:01.386292+09:00_