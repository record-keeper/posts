# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-05T08:30:01.902044+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 PSI_DRIFT_DETECTED×28 (24h)
- 🔴 CALIBRATION_DRIFT×27 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×6 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-05T08:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×30  [2026-05-05T08:00:39]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×30  [2026-05-05T08:00:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×30  [2026-05-05T08:00:39]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.2857 gap=-0.0630`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-05T06:00:07]
- key: `ROI_STAT|S00: n=110 hit%=20.9% hit_CI[Bonf]=[12.0,33.9]% ROI=0.80 ROI_boot95=[0.49,1.17]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=110<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-05T06:00:07]
- key: `ORPHAN_SCAN|95 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=110 pred=0.4298 actual=0.2091 error=+0.2207 (+51%) brier=0.2298 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🔴 CALIBRATION_DRIFT  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_DRIFT|bt=win: pred=0.4298 actual=0.2091 (+51% overconfident, n=110). EV = p * odds is `
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=110 pred=0.4298 hit=0.2091 cal_err=+0.2207 brier=0.2298 BSS=-0.39 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=10 pred=0.3276 actual=0.1000 gap=+0.2276`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=44 pred=0.4438 actual=0.2045 gap=+0.2393`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=41 pred=0.5327 actual=0.2195 gap=+0.3132`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=917 bet=300 odds=6.2 payout=390 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-05T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=931 bet=300 odds=5.9 payout=450 ratio=0.25`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.81MB / last modified 2026-05-05T08:30:03.546158+09:00

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
]: 153 combos
2026-05-05 08:27:22,506 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-05 08:28:05,785 [INFO] run_cycle: === run_cycle 08:28:05 ===
2026-05-05 08:28:05,785 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-05 08:28:05,785 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-05 08:28:05,849 [INFO] predictor: Models loaded OK
2026-05-05 08:28:06,033 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-05 08:29:05,880 [INFO] run_cycle: === run_cycle 08:29:05 ===
2026-05-05 08:29:05,880 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-05 08:29:05,880 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-05 08:29:05,924 [INFO] predictor: Models loaded OK
2026-05-05 08:29:16,965 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=23&hd=20260505: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-05 08:29:27,999 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=23&hd=20260505: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-05-05 08:29:42,362 [INFO] scraper: odds3t: 120/120 parsed
2026-05-05 08:29:43,451 [INFO] scraper: odds3f: 20/20 parsed
2026-05-05 08:29:44,580 [INFO] scraper: odds2t: 30/30 parsed
2026-05-05 08:29:44,581 [INFO] scraper: odds2f: 15/15 parsed
2026-05-05 08:29:45,656 [INFO] scraper: odds_win: 6/6 parsed
2026-05-05 08:29:45,657 [INFO] scraper: fetch_race 23/1: boats=6 odds=191/191
2026-05-05 08:29:45,668 [INFO] predictor: CALIBRATION_MODE=on
2026-05-05 08:29:45,669 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-05 08:29:45,676 [INFO] run_cycle: fetched 23/1 [final]: 156 combos
2026-05-05 08:29:45,842 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 31
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 31
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 9, 'scan': 12}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 175
  FINAL_MISSING: 51
  PSI_DRIFT_DETECTED: 28
  CALIBRATION_DRIFT: 27
  CIRCUIT_BREAKER_NO_ACTION: 17
  CIRCUIT_BREAKER_TRIP: 6
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 9 | 14,700 | 11,580 | -3,120 | 0.788 |

## 直近アラート (24h・新しい順)
```
[08:00:39] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 61, "n_recent": 49, "psi": 0.874}
[08:00:39] CALIBRATION_DRIFT: {"avg_actual": 0.1837, "avg_pred": 0.4174, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 49, "overconf_pct": 56.0}
[08:00:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 61, "n_recent": 49, "psi": 0.874}
[06:00:06] CALIBRATION_DRIFT: {"avg_actual": 0.1837, "avg_pred": 0.4174, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 49, "overconf_pct": 56.0}
[06:00:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:55:07] FINAL_MISSING: {"deadline": "2026-05-04T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050402021116", "sid": "S00"}
[23:42:06] FINAL_MISSING: {"deadline": "2026-05-04T18:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050407071810", "sid": "S00"}
[23:28:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 61, "n_recent": 49, "psi": 0.874}
[23:28:05] CALIBRATION_DRIFT: {"avg_actual": 0.1837, "avg_pred": 0.4174, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 49, "overconf_pct": 56.0}
```

## 本日残レース: 204件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 204件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 073R | win | 1 | 0.3783 | 7.6 | 2.88 | 300 | scan=9.5 drift=-20.0% | 16:18:21 |
| S00 | 011R | win | 1 | 0.4111 | 13.9 | 5.71 | 300 | scan=- drift=- | 15:15:41 |
| S00 | 166R | win | 1 | 0.5174 | 42.7 | 22.09 | 300 | scan=- drift=- | 13:27:21 |
| S00 | 1010R | win | 1 | 0.4111 | 6.1 | 2.51 | 300 | scan=4.5 drift=+35.6% | 13:02:29 |
| S00 | 2310R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=- drift=- | 12:57:46 |
| S00 | 024R | win | 1 | 0.3177 | 8.7 | 2.76 | 300 | scan=8.5 drift=+2.4% | 12:11:32 |
| S00 | 108R | win | 1 | 0.3177 | 6.5 | 2.07 | 300 | scan=6.6 drift=-1.5% | 11:56:32 |
| S00 | 021R | win | 1 | 0.4111 | 8.0 | 3.29 | 300 | scan=13.0 drift=-38.5% | 10:44:21 |
| S00 | 103R | win | 1 | 0.5174 | 8.9 | 4.60 | 300 | scan=9.0 drift=-1.1% | 09:29:22 |
| S00 | 193R | win | 1 | 0.5174 | 5.5 | 2.85 | 300 | scan=11.2 drift=-50.9% | 16:15:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 33 | -2.9% | -81.4% | +117.3% | 13 | 9 | 24 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.5s |
| **Latency** (scan→final max) | 600.7s |
| **Traffic** (notifications 24h) | 31 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 110 | 0.4298 | 0.2091 | +0.2207 | 🔴+51% | 0.2298 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 110 | 0.4298 | 0.2091 | 0.2298 | 🔴-0.39 | 0.804 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 7 | 0.2227 | 0.2857 | 🔴-0.0630 |
| 0.30-0.50 | 54 | 0.4223 | 0.1852 | 🔴+0.2371 |
| 0.50+ | 41 | 0.5327 | 0.2195 | 🔴+0.3132 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 16 | 0.61 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-05T08:30:01.902044+09:00_