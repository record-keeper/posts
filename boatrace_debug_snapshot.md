# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-25T15:30:02.074061+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×50 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×50 (24h)
- 🟡 FINAL_MISSING×50 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-25T15:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-25T15:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-10-25T15:04:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×52  [2026-10-25T15:04:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×26  [2026-10-25T15:04:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×42  [2026-10-25T14:48:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×19  [2026-10-25T12:42:51]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-25T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-25T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S00: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-25T06:00:31]
- key: `ORPHAN_SCAN|163 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-25T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-25T06:00:31]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.83 (コスト 15,700/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-25T06:00:31]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2288 actual=0.2500 gap=-0.0212`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=48.1% ROI=1.23 (コスト 7,800/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-25T06:00:31]
- key: `ROI_STAT|S00: n=186 hit%=29.6% hit_CI[Bonf]=[21.0,39.9]% ROI=0.80 ROI_boot95=[0.59,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-25T06:00:31]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=33.2% hit_CI[Bonf]=[24.3,43.5]% ROI=0.91 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-25T06:00:31]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=51.3% hit_CI[Bonf]=[35.5,66.9]% ROI=0.93 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=34.0% ROI=0.75 (コスト 11,200/回収 8,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=40.4% ROI=1.12 (コスト 20,100/回収 22,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.8MB / last modified 2026-10-25T15:30:05.038066+09:00

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
0
2026-10-25 15:28:04,935 [INFO] predictor: Models loaded OK
2026-10-25 15:28:17,588 [INFO] scraper: odds3t: 120/120 parsed
2026-10-25 15:28:18,703 [INFO] scraper: odds3f: 20/20 parsed
2026-10-25 15:28:19,860 [INFO] scraper: odds2t: 30/30 parsed
2026-10-25 15:28:19,861 [INFO] scraper: odds2f: 15/15 parsed
2026-10-25 15:28:20,938 [INFO] scraper: odds_win: 6/6 parsed
2026-10-25 15:28:20,938 [INFO] scraper: fetch_race 22/10: boats=6 odds=191/191
2026-10-25 15:28:20,941 [INFO] predictor: CALIBRATION_MODE=on
2026-10-25 15:28:20,941 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-25 15:28:20,945 [INFO] run_cycle: fetched 22/10 [scan]: 156 combos
2026-10-25 15:28:21,116 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-25 15:29:05,446 [INFO] run_cycle: === run_cycle 15:29:05 ===
2026-10-25 15:29:05,446 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-25 15:29:05,446 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-25 15:29:05,473 [INFO] predictor: Models loaded OK
2026-10-25 15:29:16,820 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=11&hd=20261025: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-25 15:29:29,249 [INFO] scraper: odds3t: 120/120 parsed
2026-10-25 15:29:30,344 [INFO] scraper: odds3f: 20/20 parsed
2026-10-25 15:29:31,463 [INFO] scraper: odds2t: 30/30 parsed
2026-10-25 15:29:31,464 [INFO] scraper: odds2f: 15/15 parsed
2026-10-25 15:29:32,557 [INFO] scraper: odds_win: 6/6 parsed
2026-10-25 15:29:32,558 [INFO] scraper: fetch_race 11/12: boats=6 odds=191/191
2026-10-25 15:29:32,561 [INFO] predictor: CALIBRATION_MODE=on
2026-10-25 15:29:32,561 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-25 15:29:32,565 [INFO] run_cycle: fetched 11/12 [scan]: 156 combos
2026-10-25 15:29:32,722 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 13, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 125
  CIRCUIT_BREAKER_TRIP: 50
  FINAL_MISSING: 50
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 12 | 12,600 | 8,190 | -4,410 | 0.65 |
| S01_NAKAANA1 | 49 | 11 | 9,800 | 4,140 | -5,660 | 0.422 |
| S02_TETSUBAN | 10 | 5 | 2,000 | 2,340 | +340 | 1.17 |

## 直近アラート (24h・新しい順)
```
[15:29:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1123}
[15:28:21] FINAL_MISSING: {"deadline": "2026-10-25T13:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102522071358", "sid": "S00"}
[15:28:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1130}
[15:27:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[15:26:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1158}
[15:25:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1152}
[15:24:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1143}
[15:23:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1160}
[15:22:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1153}
[15:21:20] FINAL_MISSING: {"deadline": "2026-10-25T13:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102508081351", "sid": "S00"}
```

## 本日残レース: 47件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 121件 締切済
- 通知発射: scan=20 nid / final=22 nid / result=10 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 0810R | win | 1 | 0.5990 | 6.6 | 3.95 | 300 | scan=29.2 drift=-77.4% | 14:46:18 |
| S01_NAKAANA1 | 089R | win | 1 | 0.5891 | 3.3 | 1.94 | 200 | scan=- drift=- | 14:17:26 |
| S00 | 226R | win | 1 | 0.4989 | 4.4 | 2.20 | 300 | scan=5.4 drift=-18.5% | 13:26:30 |
| S00 | 097R | win | 1 | 0.2290 | 4.8 | 1.10 | 300 | scan=- drift=- | 13:23:30 |
| S00 | 223R | win | 1 | 0.5891 | 9.0 | 5.30 | 300 | scan=- drift=- | 12:00:22 |
| S01_NAKAANA1 | 114R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=- drift=- | 11:48:31 |
| S00 | 174R | win | 1 | 0.5719 | 6.7 | 3.83 | 300 | scan=- drift=- | 11:42:20 |
| S00 | 041R | win | 1 | 0.4989 | 4.0 | 2.00 | 300 | scan=4.5 drift=-11.1% | 10:49:45 |
| S01_NAKAANA1 | 082R | win | 1 | 0.5686 | 3.7 | 2.10 | 200 | scan=- drift=- | 10:46:28 |
| S01_NAKAANA1 | 061R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=- drift=- | 10:39:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +15.1% | -77.4% | +369.8% | 10 | 3 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 468.8s |
| **Latency** (scan→final max) | 618.7s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 449 | 0.4810 | 0.3474 | +0.1336 | 🟡+28% | 0.2400 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4440 | 0.2973 | 0.2335 | 🔴-0.12 | 0.797 |
| S01_NAKAANA1 | win | 192 | 0.4929 | 0.3385 | 0.2398 | 🔴-0.07 | 0.901 |
| S02_TETSUBAN | win | 72 | 0.5446 | 0.5000 | 0.2572 | 🔴-0.03 | 0.869 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1854 | 0.0000 | 🔴+0.1854 |
| 0.20-0.30 | 9 | 0.2288 | 0.2222 | ✅+0.0066 |
| 0.30-0.50 | 153 | 0.4117 | 0.3007 | 🔴+0.1111 |
| 0.50+ | 274 | 0.5435 | 0.3869 | 🔴+0.1566 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 192 | 0.781 |
| win | <5.0 | ✅learned | 351 | 0.741 |
| win | <10.0 | ✅learned | 154 | 0.452 |
| win | <20.0 | ✅learned | 43 | 0.254 |
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
_auto-generated by claude_snapshot.py at 2026-10-25T15:30:02.074061+09:00_